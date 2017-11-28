---
title: "Tutorial: Integración de Azure Active Directory con Skydesk Email | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y el correo electrónico de SkyDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="bdafc-103">Tutorial: Integración de Azure Active Directory con Skydesk Email</span><span class="sxs-lookup"><span data-stu-id="bdafc-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>

<span data-ttu-id="bdafc-104">En este tutorial, aprenderá cómo toointegrate SkyDesk de correo electrónico con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bdafc-104">In this tutorial, you learn how toointegrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdafc-105">Integración de correo electrónico de SkyDesk con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bdafc-105">Integrating SkyDesk Email with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bdafc-106">Puede controlar en Azure AD que tenga acceso tooSkyDesk correo electrónico</span><span class="sxs-lookup"><span data-stu-id="bdafc-106">You can control in Azure AD who has access tooSkyDesk Email</span></span>
- <span data-ttu-id="bdafc-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooSkyDesk correo electrónico (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdafc-107">You can enable your users tooautomatically get signed-on tooSkyDesk Email (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bdafc-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bdafc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bdafc-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bdafc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdafc-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bdafc-110">Prerequisites</span></span>

<span data-ttu-id="bdafc-111">integración de Azure AD con correo electrónico de SkyDesk tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="bdafc-111">tooconfigure Azure AD integration with SkyDesk Email, you need hello following items:</span></span>

- <span data-ttu-id="bdafc-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdafc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdafc-113">Una suscripción habilitada para el inicio de sesión único en Skydesk Email</span><span class="sxs-lookup"><span data-stu-id="bdafc-113">A SkyDesk Email single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdafc-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="bdafc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdafc-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="bdafc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdafc-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bdafc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdafc-117">Si no dispone de un entorno de prueba de Azure AD, aquí puede obtener una versión de prueba de un mes [oferta de prueba](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bdafc-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdafc-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="bdafc-118">Scenario description</span></span>
<span data-ttu-id="bdafc-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="bdafc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdafc-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="bdafc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdafc-121">Agregar correo electrónico SkyDesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bdafc-121">Adding SkyDesk Email from hello gallery</span></span>
2. <span data-ttu-id="bdafc-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdafc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skydesk-email-from-hello-gallery"></a><span data-ttu-id="bdafc-123">Agregar correo electrónico SkyDesk desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="bdafc-123">Adding SkyDesk Email from hello gallery</span></span>
<span data-ttu-id="bdafc-124">integración de hello tooconfigure SkyDesk el correo electrónico en Azure AD, deberá tooadd correo electrónico SkyDesk de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="bdafc-124">tooconfigure hello integration of SkyDesk Email into Azure AD, you need tooadd SkyDesk Email from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bdafc-125">**tooadd correo electrónico SkyDesk desde la Galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bdafc-125">**tooadd SkyDesk Email from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdafc-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bdafc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bdafc-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bdafc-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-129">Then go too**All applications**.</span></span>

    ![Aplicaciones][2]
    
3. <span data-ttu-id="bdafc-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bdafc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicaciones][3]

4. <span data-ttu-id="bdafc-133">En el cuadro de búsqueda de hello, escriba **correo electrónico SkyDesk**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-133">In hello search box, type **SkyDesk Email**.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. <span data-ttu-id="bdafc-135">En el panel de resultados de hello, seleccione **correo electrónico SkyDesk**y, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bdafc-135">In hello results panel, select **SkyDesk Email**, and then click **Add** button tooadd hello application.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bdafc-137">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdafc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bdafc-138">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con SkyDesk Email utilizando un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bdafc-138">In this section, you configure and test Azure AD single sign-on with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bdafc-139">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en correo electrónico de SkyDesk es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bdafc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SkyDesk Email is tooa user in Azure AD.</span></span> <span data-ttu-id="bdafc-140">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en correo electrónico de SkyDesk debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="bdafc-140">In other words, a link relationship between an Azure AD user and hello related user in SkyDesk Email needs toobe established.</span></span>

<span data-ttu-id="bdafc-141">En correo electrónico de SkyDesk, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdafc-141">In SkyDesk Email, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bdafc-142">tooconfigure y prueba de inicio de sesión único en Azure AD con correo electrónico SkyDesk, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="bdafc-142">tooconfigure and test Azure AD single sign-on with SkyDesk Email, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bdafc-143">**[Configuración de Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="bdafc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bdafc-144">**[Crear un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bdafc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdafc-145">**[Crear un usuario de prueba de correo electrónico de SkyDesk](#creating-a-skydesk-email-test-user)**  -toohave un equivalente de Britta Simon en correo electrónico SkyDesk representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="bdafc-145">**[Creating a SkyDesk Email test user](#creating-a-skydesk-email-test-user)** - toohave a counterpart of Britta Simon in SkyDesk Email that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bdafc-146">**[Asignar usuario de prueba de hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bdafc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdafc-147">**[Pruebas de Single Sign-On](#testing-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="bdafc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bdafc-148">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdafc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bdafc-149">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación de correo electrónico SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="bdafc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="bdafc-150">**inicio de sesión único en tooconfigure Azure AD con correo electrónico SkyDesk realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bdafc-150">**tooconfigure Azure AD single sign-on with SkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdafc-151">En el portal de Azure, en Hola Hola **correo electrónico SkyDesk** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-151">In hello Azure portal, on hello **SkyDesk Email** application integration page, click **Single sign-on**.</span></span>

    ![Configurar inicio de sesión único][4]

2. <span data-ttu-id="bdafc-153">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="bdafc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. <span data-ttu-id="bdafc-155">En hello **SkyDesk dominio de correo electrónico y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bdafc-155">On hello **SkyDesk Email Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    <span data-ttu-id="bdafc-157">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://mail.skydesk.jp/portal/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="bdafc-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.skydesk.jp/portal/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bdafc-158">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="bdafc-158">hello value is not real.</span></span> <span data-ttu-id="bdafc-159">Valor de Hola de actualización con Hola dirección URL de inicio de sesión real.</span><span class="sxs-lookup"><span data-stu-id="bdafc-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="bdafc-160">Póngase en contacto con [equipo de soporte técnico de cliente de correo electrónico de SkyDesk](https://www.skydesk.sg/support/) tooget valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdafc-160">Contact [SkyDesk Email Client support team](https://www.skydesk.sg/support/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="bdafc-161">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="bdafc-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. <span data-ttu-id="bdafc-163">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="bdafc-163">Click **Save** button.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bdafc-165">En hello **configuración de correo electrónico de SkyDesk** sección, haga clic en **configurar correo electrónico de SkyDesk** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="bdafc-165">On hello **SkyDesk Email Configuration** section, click **Configure SkyDesk Email** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bdafc-166">Hola copia **dirección URL de cierre de sesión y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="bdafc-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. <span data-ttu-id="bdafc-168">tooenable SSO en **correo electrónico SkyDesk**, realizar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bdafc-168">tooenable SSO in **SkyDesk Email**, perform hello following steps:</span></span>

    <span data-ttu-id="bdafc-169">a.</span><span class="sxs-lookup"><span data-stu-id="bdafc-169">a.</span></span> <span data-ttu-id="bdafc-170">Inicio de sesión tooyour cuenta de correo electrónico de SkyDesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="bdafc-170">Sign-on tooyour SkyDesk Email account as administrator.</span></span>

    <span data-ttu-id="bdafc-171">b.</span><span class="sxs-lookup"><span data-stu-id="bdafc-171">b.</span></span> <span data-ttu-id="bdafc-172">En el menú de hello en la parte superior de hello, haga clic en **el programa de instalación**y seleccione **Org**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-172">In hello menu on hello top, click **Setup**, and select **Org**.</span></span> 
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    <span data-ttu-id="bdafc-174">c.</span><span class="sxs-lookup"><span data-stu-id="bdafc-174">c.</span></span> <span data-ttu-id="bdafc-175">Haga clic en **dominios** desde el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdafc-175">Click on **Domains** from hello left panel.</span></span>
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    <span data-ttu-id="bdafc-177">d.</span><span class="sxs-lookup"><span data-stu-id="bdafc-177">d.</span></span> <span data-ttu-id="bdafc-178">Haga clic en **Add Domain** (Agregar dominio).</span><span class="sxs-lookup"><span data-stu-id="bdafc-178">Click on **Add Domain**.</span></span>
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    <span data-ttu-id="bdafc-180">e.</span><span class="sxs-lookup"><span data-stu-id="bdafc-180">e.</span></span> <span data-ttu-id="bdafc-181">Escriba el nombre de dominio y, a continuación, compruebe Hola dominio.</span><span class="sxs-lookup"><span data-stu-id="bdafc-181">Enter your Domain name, and then verify hello Domain.</span></span>
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    <span data-ttu-id="bdafc-183">f.</span><span class="sxs-lookup"><span data-stu-id="bdafc-183">f.</span></span> <span data-ttu-id="bdafc-184">Haga clic en **autenticación SAML** desde el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdafc-184">Click on **SAML Authentication** from hello left panel.</span></span>
    
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. <span data-ttu-id="bdafc-186">En hello **autenticación SAML** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bdafc-186">On hello **SAML Authentication** dialog page, perform hello following steps:</span></span>
   
      ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="bdafc-188">autenticación basada en toouse SAML, o bien debe tener **comprobado dominio** o **portal URL** el programa de instalación.</span><span class="sxs-lookup"><span data-stu-id="bdafc-188">toouse SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="bdafc-189">Puede establecer el portal de hello dirección URL con el nombre único de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdafc-189">You can set hello portal URL with hello unique name.</span></span>
    > 
    > 
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    <span data-ttu-id="bdafc-191">a.</span><span class="sxs-lookup"><span data-stu-id="bdafc-191">a.</span></span> <span data-ttu-id="bdafc-192">Hola **dirección URL de inicio de sesión** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bdafc-192">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="bdafc-193">b.</span><span class="sxs-lookup"><span data-stu-id="bdafc-193">b.</span></span> <span data-ttu-id="bdafc-194">Hola **Logout** cuadro de texto de dirección URL, pegar Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bdafc-194">In hello **Logout** URL textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bdafc-195">c.</span><span class="sxs-lookup"><span data-stu-id="bdafc-195">c.</span></span> <span data-ttu-id="bdafc-196">**Cambiar dirección URL de contraseña** es opcional, déjelo en blanco.</span><span class="sxs-lookup"><span data-stu-id="bdafc-196">**Change Password URL** is optional so leave it blank.</span></span>

    <span data-ttu-id="bdafc-197">d.</span><span class="sxs-lookup"><span data-stu-id="bdafc-197">d.</span></span> <span data-ttu-id="bdafc-198">Haga clic en **obtener clave de archivo** tooselect el certificado descargado del portal de Azure y, a continuación, haga clic en **abiertos** certificado de hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="bdafc-198">Click on **Get Key From File** tooselect your downloaded certificate from Azure portal, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="bdafc-199">e.</span><span class="sxs-lookup"><span data-stu-id="bdafc-199">e.</span></span> <span data-ttu-id="bdafc-200">En **Algoritmo**, seleccione **RSA**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-200">As **Algorithm**, select **RSA**.</span></span>

    <span data-ttu-id="bdafc-201">f.</span><span class="sxs-lookup"><span data-stu-id="bdafc-201">f.</span></span> <span data-ttu-id="bdafc-202">Haga clic en **Aceptar** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="bdafc-202">Click **Ok** toosave hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="bdafc-203">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="bdafc-203">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bdafc-204">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="bdafc-204">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bdafc-205">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdafc-205">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bdafc-206">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdafc-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="bdafc-207">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="bdafc-207">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de Azure AD][100]

<span data-ttu-id="bdafc-209">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bdafc-209">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdafc-210">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="bdafc-210">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bdafc-212">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-212">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bdafc-214">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdafc-214">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bdafc-216">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="bdafc-216">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bdafc-218">a.</span><span class="sxs-lookup"><span data-stu-id="bdafc-218">a.</span></span> <span data-ttu-id="bdafc-219">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-219">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdafc-220">b.</span><span class="sxs-lookup"><span data-stu-id="bdafc-220">b.</span></span> <span data-ttu-id="bdafc-221">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bdafc-221">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bdafc-222">c.</span><span class="sxs-lookup"><span data-stu-id="bdafc-222">c.</span></span> <span data-ttu-id="bdafc-223">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-223">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bdafc-224">d.</span><span class="sxs-lookup"><span data-stu-id="bdafc-224">d.</span></span> <span data-ttu-id="bdafc-225">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-225">Click **Create**.</span></span>
 
### <a name="creating-a-skydesk-email-test-user"></a><span data-ttu-id="bdafc-226">Creación de un usuario de prueba de Skydesk Email</span><span class="sxs-lookup"><span data-stu-id="bdafc-226">Creating a SkyDesk Email test user</span></span>

<span data-ttu-id="bdafc-227">En esta sección, creará un usuario llamado Britta Simon en Skydesk Email.</span><span class="sxs-lookup"><span data-stu-id="bdafc-227">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="bdafc-228">Haga clic en **acceso de usuario** de hello izquierda del panel de correo electrónico de SkyDesk y, a continuación, escriba el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="bdafc-228">Click on **User Access** from hello left panel in SkyDesk Email and then enter your username.</span></span> 

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="bdafc-230">Si necesita que los usuarios de forma masiva toocreate, necesita hello toocontact [equipo de soporte técnico de cliente de correo electrónico de SkyDesk](https://www.skydesk.sg/support/).</span><span class="sxs-lookup"><span data-stu-id="bdafc-230">If you need toocreate bulk users, you need toocontact hello [SkyDesk Email Client support team](https://www.skydesk.sg/support/).</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bdafc-231">Asignación de usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bdafc-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bdafc-232">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooSkyDesk correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="bdafc-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkyDesk Email.</span></span>

![Asignar usuario][200] 

<span data-ttu-id="bdafc-234">**tooassign Britta Simon tooSkyDesk de correo electrónico, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="bdafc-234">**tooassign Britta Simon tooSkyDesk Email, perform hello following steps:**</span></span>

1. <span data-ttu-id="bdafc-235">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="bdafc-237">En la lista de aplicaciones de hello, seleccione **correo electrónico SkyDesk**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-237">In hello applications list, select **SkyDesk Email**.</span></span>

    ![Configurar inicio de sesión único](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. <span data-ttu-id="bdafc-239">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Asignar usuario][202] 

4. <span data-ttu-id="bdafc-241">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-241">Click **Add** button.</span></span> <span data-ttu-id="bdafc-242">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Asignar usuario][203]

5. <span data-ttu-id="bdafc-244">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bdafc-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bdafc-245">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdafc-246">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="bdafc-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bdafc-247">Prueba del inicio de sesión único </span><span class="sxs-lookup"><span data-stu-id="bdafc-247">Testing single sign-on</span></span>

<span data-ttu-id="bdafc-248">objetivo de Hola de esta sección es tootest la configuración de SSO de Azure AD mediante Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="bdafc-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="bdafc-249">Al hacer clic en hello correo electrónico SkyDesk el icono Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour aplicación de correo electrónico SkyDesk.</span><span class="sxs-lookup"><span data-stu-id="bdafc-249">When you click hello SkyDesk Email tile in hello Access Panel, you should get automatically signed-on tooyour SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bdafc-250">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="bdafc-250">Additional resources</span></span>

* [<span data-ttu-id="bdafc-251">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdafc-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdafc-252">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bdafc-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png


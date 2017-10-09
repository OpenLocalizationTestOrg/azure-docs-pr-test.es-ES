---
title: "Tutorial: Integración de Azure Active Directory con Workstars | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a><span data-ttu-id="fbc6a-103">Tutorial: integración de Azure Active Directory con Workstars</span><span class="sxs-lookup"><span data-stu-id="fbc6a-103">Tutorial: Azure Active Directory integration with Workstars</span></span>

<span data-ttu-id="fbc6a-104">En este tutorial, aprenderá cómo toointegrate Workstars con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbc6a-104">In this tutorial, you learn how toointegrate Workstars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbc6a-105">Integración Workstars con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="fbc6a-105">Integrating Workstars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fbc6a-106">Puede controlar en Azure AD que tenga acceso tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-106">You can control in Azure AD who has access tooWorkstars.</span></span>
- <span data-ttu-id="fbc6a-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooWorkstars (Single Sign-On) con sus cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-107">You can enable your users tooautomatically get signed-on tooWorkstars (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fbc6a-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="fbc6a-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbc6a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbc6a-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fbc6a-110">Prerequisites</span></span>

<span data-ttu-id="fbc6a-111">integración de Azure AD con Workstars tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="fbc6a-111">tooconfigure Azure AD integration with Workstars, you need hello following items:</span></span>

- <span data-ttu-id="fbc6a-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbc6a-113">Una suscripción habilitada para el inicio de sesión único en Workstars</span><span class="sxs-lookup"><span data-stu-id="fbc6a-113">A Workstars single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbc6a-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbc6a-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="fbc6a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbc6a-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbc6a-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbc6a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbc6a-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="fbc6a-118">Scenario description</span></span>
<span data-ttu-id="fbc6a-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbc6a-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="fbc6a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbc6a-121">Agregar Workstars desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fbc6a-121">Adding Workstars from hello gallery</span></span>
2. <span data-ttu-id="fbc6a-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc6a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workstars-from-hello-gallery"></a><span data-ttu-id="fbc6a-123">Agregar Workstars desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="fbc6a-123">Adding Workstars from hello gallery</span></span>
<span data-ttu-id="fbc6a-124">integración de hello tooconfigure de Workstars en Azure AD, deberá tooadd Workstars de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-124">tooconfigure hello integration of Workstars into Azure AD, you need tooadd Workstars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fbc6a-125">**tooadd Workstars de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fbc6a-125">**tooadd Workstars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbc6a-126">Hola  **[portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="fbc6a-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fbc6a-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="fbc6a-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="fbc6a-133">En el cuadro de búsqueda de hello, escriba **Workstars**, seleccione **Workstars** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-133">In hello search box, type **Workstars**, select **Workstars** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workstars en la lista de resultados de Hola](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fbc6a-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc6a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fbc6a-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Workstars con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fbc6a-136">In this section, you configure and test Azure AD single sign-on with Workstars based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbc6a-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Workstars es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workstars is tooa user in Azure AD.</span></span> <span data-ttu-id="fbc6a-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Workstars debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-138">In other words, a link relationship between an Azure AD user and hello related user in Workstars needs toobe established.</span></span>

<span data-ttu-id="fbc6a-139">En Workstars, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-139">In Workstars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fbc6a-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Workstars, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="fbc6a-140">tooconfigure and test Azure AD single sign-on with Workstars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fbc6a-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fbc6a-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**  -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbc6a-143">**[Crear un usuario de prueba Workstars](#create-a-workstars-test-user)**  -toohave un equivalente de Britta Simon en Workstars que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-143">**[Create a Workstars test user](#create-a-workstars-test-user)** - toohave a counterpart of Britta Simon in Workstars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbc6a-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbc6a-145">**[Probar el inicio de sesión único](#test-single-sign-on)**  -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fbc6a-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc6a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fbc6a-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Workstars.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workstars application.</span></span>

<span data-ttu-id="fbc6a-148">**inicio de sesión único en Azure AD tooconfigure con Workstars, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fbc6a-148">**tooconfigure Azure AD single sign-on with Workstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbc6a-149">En el portal de Azure, en Hola Hola **Workstars** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-149">In hello Azure portal, on hello **Workstars** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="fbc6a-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. <span data-ttu-id="fbc6a-153">En hello **Workstars dominio y las direcciones URL** sección, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fbc6a-153">On hello **Workstars Domain and URLs** section, perform hello following steps:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    <span data-ttu-id="fbc6a-155">a.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-155">a.</span></span> <span data-ttu-id="fbc6a-156">Hola **identificador** cuadro de texto, escriba la dirección URL hello:`https://workstars.com`</span><span class="sxs-lookup"><span data-stu-id="fbc6a-156">In hello **Identifier** textbox, type hello URL: `https://workstars.com`</span></span>

    <span data-ttu-id="fbc6a-157">b.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-157">b.</span></span> <span data-ttu-id="fbc6a-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<subdomain>.workstars.com/saml/login_check`</span><span class="sxs-lookup"><span data-stu-id="fbc6a-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.workstars.com/saml/login_check`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fbc6a-159">valor de Hello no es real.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-159">hello value is not real.</span></span> <span data-ttu-id="fbc6a-160">Valor de Hola de actualización con Hola dirección URL de respuesta real.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-160">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="fbc6a-161">Póngase en contacto con [equipo de soporte técnico Workstars](https://support.workstars.com) valor de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-161">Contact [Workstars support team](https://support.workstars.com) tooget hello value.</span></span>
 
4. <span data-ttu-id="fbc6a-162">En hello **el certificado de firma de SAML** sección, haga clic en **certificado (Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. <span data-ttu-id="fbc6a-164">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="fbc6a-164">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbc6a-166">En hello **Workstars configuración** sección, haga clic en **configurar Workstars** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-166">On hello **Workstars Configuration** section, click **Configure Workstars** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="fbc6a-167">Hola copia **dirección URL de cierre de sesión, Id. de entidad de SAML y SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="fbc6a-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. <span data-ttu-id="fbc6a-169">En otra ventana del explorador, inicie sesión en el sitio de empresa de tooyour Workstars como administrador.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-169">In another browser window, sign on tooyour Workstars company site as an administrator.</span></span>

8. <span data-ttu-id="fbc6a-170">En la barra de herramientas principal de hello, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-170">In hello main toolbar, click **Settings**.</span></span>

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. <span data-ttu-id="fbc6a-172">Vaya demasiado**inicio de sesión** > **configuración**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-172">Go too**Sign On** > **Settings**.</span></span>

    ![Inicio de sesión de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Configuración de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. <span data-ttu-id="fbc6a-175">En hello **único inicio de sesión en (SAML) - configuración** , siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="fbc6a-175">On hello **Single Sign On (SAML) - Settings** page, perform hello following steps:</span></span>
    
    ![SAML de Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    <span data-ttu-id="fbc6a-177">a.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-177">a.</span></span> <span data-ttu-id="fbc6a-178">En el cuadro de texto **Nombre del proveedor de identidad**, escriba **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-178">In **Identity Provider Name** textbox, type **Office 365**.</span></span>

    <span data-ttu-id="fbc6a-179">b.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-179">b.</span></span> <span data-ttu-id="fbc6a-180">Hola **Id. de entidad de proveedor de identidad** cuadro de texto, pegue Hola valo **Id. de entidad SAML**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-180">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="fbc6a-181">c.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-181">c.</span></span> <span data-ttu-id="fbc6a-182">Copie el contenido de Hola Hola descargado del archivo de certificado en el Bloc de notas y, a continuación, péguelo en hello **x509 certificado** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-182">Copy hello content of hello downloaded certificate file in notepad, and then paste it into hello **x509 Certificate** textbox.</span></span> 

    <span data-ttu-id="fbc6a-183">d.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-183">d.</span></span> <span data-ttu-id="fbc6a-184">Hola **dirección URL SSO SAML** cuadro de texto, pegue Hola valo **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-184">In hello **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="fbc6a-185">e.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-185">e.</span></span> <span data-ttu-id="fbc6a-186">Hola **dirección URL de cierre de sesión remoto** cuadro de texto, pegue Hola valo **dirección URL de cierre de sesión**, que haya copiado desde el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-186">In hello **Remote Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="fbc6a-187">f.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-187">f.</span></span> <span data-ttu-id="fbc6a-188">Seleccione **Id. de nombre** como **Correo electrónico (predeterminado)**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-188">select **Name ID** as **Email (Default)**.</span></span>

    <span data-ttu-id="fbc6a-189">g.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-189">g.</span></span> <span data-ttu-id="fbc6a-190">Haga clic en **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-190">Click **Confirm**.</span></span>
    
> [!TIP]
> <span data-ttu-id="fbc6a-191">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="fbc6a-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fbc6a-192">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello  **Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fbc6a-193">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbc6a-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fbc6a-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc6a-194">Create an Azure AD test user</span></span>

<span data-ttu-id="fbc6a-195">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="fbc6a-197">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fbc6a-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbc6a-198">Hola portal de Azure, en el panel izquierdo de hello, haga clic en hello **Azure Active Directory** botón.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-198">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="fbc6a-200">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos**y, a continuación, haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-200">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="fbc6a-202">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en parte superior de Hola de hello **todos los usuarios** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-202">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botón de agregar Hola](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="fbc6a-204">Hola **usuario** diálogo cuadro, lleve a cabo Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="fbc6a-204">In hello **User** dialog box, perform hello following steps:</span></span>

    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fbc6a-206">a.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-206">a.</span></span> <span data-ttu-id="fbc6a-207">Hola **nombre** , escriba **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-207">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbc6a-208">b.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-208">b.</span></span> <span data-ttu-id="fbc6a-209">Hola **nombre de usuario** cuadro de dirección de correo electrónico de tipo hello del usuario Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-209">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="fbc6a-210">c.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-210">c.</span></span> <span data-ttu-id="fbc6a-211">Seleccione hello **Mostrar contraseña** casilla de verificación y, a continuación, anote el valor de Hola que se muestra en hello **contraseña** cuadro.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-211">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="fbc6a-212">d.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-212">d.</span></span> <span data-ttu-id="fbc6a-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-213">Click **Create**.</span></span>
  
### <a name="create-a-workstars-test-user"></a><span data-ttu-id="fbc6a-214">Creación de un usuario de prueba de Workstars</span><span class="sxs-lookup"><span data-stu-id="fbc6a-214">Create a Workstars test user</span></span>

<span data-ttu-id="fbc6a-215">En esta sección, se crea un usuario denominado Britta Simon en Workstars.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-215">In this section, you create a user called Britta Simon in Workstars.</span></span> <span data-ttu-id="fbc6a-216">Trabajar con [equipo de soporte técnico Workstars](https://support.workstars.com) a los usuarios de tooadd hello en la plataforma de Workstars Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-216">Work with [Workstars support team](https://support.workstars.com) tooadd hello users in hello Workstars platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="fbc6a-217">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbc6a-217">Assign hello Azure AD test user</span></span>

<span data-ttu-id="fbc6a-218">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooWorkstars.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkstars.</span></span>

![Asigne el rol de usuario de Hola][200] 

<span data-ttu-id="fbc6a-220">**tooassign Britta Simon tooWorkstars, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="fbc6a-220">**tooassign Britta Simon tooWorkstars, perform hello following steps:**</span></span>

1. <span data-ttu-id="fbc6a-221">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="fbc6a-223">En la lista de aplicaciones de hello, seleccione **Workstars**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-223">In hello applications list, select **Workstars**.</span></span>

    ![vínculo de Workstars Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. <span data-ttu-id="fbc6a-225">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="fbc6a-227">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-227">Click **Add** button.</span></span> <span data-ttu-id="fbc6a-228">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="fbc6a-230">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fbc6a-231">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbc6a-232">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="fbc6a-233">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="fbc6a-233">Test single sign-on</span></span>

<span data-ttu-id="fbc6a-234">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="fbc6a-235">Al hacer clic en hello Workstars el icono Panel de acceso de hello, debería obtener automáticamente ha iniciado sesión tooyour Workstars aplicación.</span><span class="sxs-lookup"><span data-stu-id="fbc6a-235">When you click hello Workstars tile in hello Access Panel, you should get automatically signed-on tooyour Workstars application.</span></span>
<span data-ttu-id="fbc6a-236">Para obtener más información sobre el Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbc6a-236">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fbc6a-237">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="fbc6a-237">Additional resources</span></span>

* [<span data-ttu-id="fbc6a-238">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbc6a-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbc6a-239">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fbc6a-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png


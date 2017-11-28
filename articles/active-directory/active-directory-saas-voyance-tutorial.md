---
title: "Tutorial: Integración de Azure Active Directory con Voyance | Microsoft Docs"
description: "Obtenga información acerca de cómo tooconfigure inicio de sesión único entre Azure Active Directory y Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e2cb9eb6b20e8611a9f6e8529b7c85a8d86ec3e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="458f1-103">Tutorial: Integración de Azure Active Directory con Voyance</span><span class="sxs-lookup"><span data-stu-id="458f1-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="458f1-104">En este tutorial, aprenderá cómo toointegrate Voyance con Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="458f1-104">In this tutorial, you learn how toointegrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="458f1-105">Integración Voyance con Azure AD proporciona Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="458f1-105">Integrating Voyance with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="458f1-106">Puede controlar en Azure AD que tenga acceso tooVoyance</span><span class="sxs-lookup"><span data-stu-id="458f1-106">You can control in Azure AD who has access tooVoyance</span></span>
- <span data-ttu-id="458f1-107">Puede habilitar los usuarios tooautomatically get ha iniciado sesión tooVoyance (Single Sign-On) con sus cuentas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="458f1-107">You can enable your users tooautomatically get signed-on tooVoyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="458f1-108">Puede administrar las cuentas en una ubicación central: Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="458f1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="458f1-109">Si desea obtener más información acerca de la integración de aplicaciones de SaaS con Azure AD tooknow, consulte [¿qué es acceso a la aplicación y el inicio de sesión único con Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="458f1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="458f1-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="458f1-110">Prerequisites</span></span>

<span data-ttu-id="458f1-111">integración de Azure AD con Voyance tooconfigure, necesita Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="458f1-111">tooconfigure Azure AD integration with Voyance, you need hello following items:</span></span>

- <span data-ttu-id="458f1-112">Una suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="458f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="458f1-113">Una suscripción habilitada para el inicio de sesión único en Voyance</span><span class="sxs-lookup"><span data-stu-id="458f1-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="458f1-114">Hola tootest los pasos de este tutorial, no se recomienda usar un entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="458f1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="458f1-115">pasos de hello tootest en este tutorial, debe seguir estas recomendaciones:</span><span class="sxs-lookup"><span data-stu-id="458f1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="458f1-116">No use el entorno de producción, salvo que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="458f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="458f1-117">Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="458f1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="458f1-118">Descripción del escenario</span><span class="sxs-lookup"><span data-stu-id="458f1-118">Scenario description</span></span>
<span data-ttu-id="458f1-119">En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba.</span><span class="sxs-lookup"><span data-stu-id="458f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="458f1-120">escenario de Hello descrito en este tutorial consta de dos bloques principales:</span><span class="sxs-lookup"><span data-stu-id="458f1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="458f1-121">Agregar Voyance desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="458f1-121">Adding Voyance from hello gallery</span></span>
2. <span data-ttu-id="458f1-122">Configuración y comprobación del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="458f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-hello-gallery"></a><span data-ttu-id="458f1-123">Agregar Voyance desde la Galería de Hola</span><span class="sxs-lookup"><span data-stu-id="458f1-123">Adding Voyance from hello gallery</span></span>
<span data-ttu-id="458f1-124">integración de hello tooconfigure de Voyance en Azure AD, deberá tooadd Voyance de lista de tooyour Hola Galería de aplicaciones administradas de SaaS.</span><span class="sxs-lookup"><span data-stu-id="458f1-124">tooconfigure hello integration of Voyance into Azure AD, you need tooadd Voyance from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="458f1-125">**tooadd Voyance de galería de hello, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="458f1-125">**tooadd Voyance from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="458f1-126">Hola ** [portal de Azure](https://portal.azure.com)**, en el panel de navegación izquierdo de Hola, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="458f1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botón de Hello Azure Active Directory][1]

2. <span data-ttu-id="458f1-128">Navegue demasiado**aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="458f1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="458f1-129">A continuación, vaya demasiado**todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="458f1-129">Then go too**All applications**.</span></span>

    ![hoja de aplicaciones de empresa de Hola][2]
    
3. <span data-ttu-id="458f1-131">tooadd nueva aplicación, haga clic en **nueva aplicación** botón en la parte superior de saludo del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="458f1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![botón de nueva aplicación Hola][3]

4. <span data-ttu-id="458f1-133">En el cuadro de búsqueda de hello, escriba **Voyance**, seleccione **Voyance** desde el panel de resultados, a continuación, haga clic en **agregar** botón aplicación hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="458f1-133">In hello search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Voyance en la lista de resultados de Hola](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="458f1-135">Configuración y prueba del inicio de sesión único en Azure AD</span><span class="sxs-lookup"><span data-stu-id="458f1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="458f1-136">En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Voyance con un usuario de prueba llamado "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="458f1-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="458f1-137">Para toowork de inicio de sesión único, Azure AD necesita tooknow qué usuario equivalente de hello en Voyance es tooa usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="458f1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Voyance is tooa user in Azure AD.</span></span> <span data-ttu-id="458f1-138">En otras palabras, una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de hello en Voyance debe toobe establecido.</span><span class="sxs-lookup"><span data-stu-id="458f1-138">In other words, a link relationship between an Azure AD user and hello related user in Voyance needs toobe established.</span></span>

<span data-ttu-id="458f1-139">En Voyance, asigne el valor de Hola de hello **nombre de usuario** en Azure AD como valor de Hola de hello **nombre de usuario** tooestablish la relación de vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="458f1-139">In Voyance, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="458f1-140">tooconfigure y prueba de inicio de sesión único en Azure AD con Voyance, deberá hello toocomplete después de bloques de creación:</span><span class="sxs-lookup"><span data-stu-id="458f1-140">tooconfigure and test Azure AD single sign-on with Voyance, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="458f1-141">**[Configurar Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable la toouse usuarios esta característica.</span><span class="sxs-lookup"><span data-stu-id="458f1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="458f1-142">**[Crear un usuario de prueba de Azure AD](#create-an-azure-ad-test-user) ** -inicio de sesión único en Azure AD tootest con Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="458f1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="458f1-143">**[Crear un usuario de prueba Voyance](#create-a-voyance-test-user) ** -toohave un equivalente de Britta Simon en Voyance que es la representación toohello vinculado Azure AD del usuario.</span><span class="sxs-lookup"><span data-stu-id="458f1-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - toohave a counterpart of Britta Simon in Voyance that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="458f1-144">**[Asignar el usuario de prueba de hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="458f1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="458f1-145">**[Probar el inicio de sesión único](#test-single-sign-on) ** -tooverify Hola si funciona la configuración.</span><span class="sxs-lookup"><span data-stu-id="458f1-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="458f1-146">Configuración del inicio de sesión único de Azure AD</span><span class="sxs-lookup"><span data-stu-id="458f1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="458f1-147">En esta sección, habilitar inicio de sesión único en Azure AD en hello portal de Azure y configurar el inicio de sesión único en la aplicación Voyance.</span><span class="sxs-lookup"><span data-stu-id="458f1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="458f1-148">**inicio de sesión único en Azure AD tooconfigure con Voyance, realizar Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="458f1-148">**tooconfigure Azure AD single sign-on with Voyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="458f1-149">En el portal de Azure, en Hola Hola **Voyance** página de integración de aplicaciones, haga clic en **inicio de sesión único**.</span><span class="sxs-lookup"><span data-stu-id="458f1-149">In hello Azure portal, on hello **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Vínculo Configurar inicio de sesión único][4]

2. <span data-ttu-id="458f1-151">En hello **inicio de sesión único** cuadro de diálogo, seleccione **modo** como **sesión basado en SAML** tooenable inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="458f1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Cuadro de diálogo Inicio de sesión único](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="458f1-153">En hello **Voyance dominio y las direcciones URL** sección, lleve a cabo Hola siguientes pasos si desea tooconfigure aplicación de hello en **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="458f1-153">On hello **Voyance Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Voyance para IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="458f1-155">a.</span><span class="sxs-lookup"><span data-stu-id="458f1-155">a.</span></span> <span data-ttu-id="458f1-156">Hola **identificador** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="458f1-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="458f1-157">b.</span><span class="sxs-lookup"><span data-stu-id="458f1-157">b.</span></span> <span data-ttu-id="458f1-158">Hola **dirección URL de respuesta** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="458f1-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="458f1-159">Comprobar **mostrar avanzadas de configuración de direcciones URL** y realizar Hola siguiendo el paso si desea tooconfigure aplicación de hello en **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="458f1-159">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Información de dominio y direcciones URL de inicio de sesión único de Voyance para SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="458f1-161">Hola **dirección URL de inicio de sesión** cuadro de texto, escriba una dirección URL usando Hola siguiente patrón:`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="458f1-161">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="458f1-162">Estos valores no son reales.</span><span class="sxs-lookup"><span data-stu-id="458f1-162">These values are not real.</span></span> <span data-ttu-id="458f1-163">Actualizar estos valores con hello real identificador, dirección URL de respuesta y dirección URL de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="458f1-163">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="458f1-164">Póngase en contacto con [equipo de soporte técnico de cliente de Voyance](mailto:support@nyansa.com) tooget estos valores.</span><span class="sxs-lookup"><span data-stu-id="458f1-164">Contact [Voyance Client support team](mailto:support@nyansa.com) tooget these values.</span></span> 

5. <span data-ttu-id="458f1-165">En hello **el certificado de firma de SAML** sección, haga clic en **Certificate(Base64)** y, a continuación, guarde el archivo de certificado de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="458f1-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![vínculo de descarga del certificado de Hola](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="458f1-167">Haga clic en el botón **Guardar** .</span><span class="sxs-lookup"><span data-stu-id="458f1-167">Click **Save** button.</span></span>

    ![Botón Guardar de Configuración de inicio de sesión único](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="458f1-169">En hello **Voyance configuración** sección, haga clic en **configurar Voyance** tooopen **configurar inicio de sesión** ventana.</span><span class="sxs-lookup"><span data-stu-id="458f1-169">On hello **Voyance Configuration** section, click **Configure Voyance** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="458f1-170">Hola copia **SAML Single Sign-On dirección URL del servicio** de hello **sección de referencia rápida.**</span><span class="sxs-lookup"><span data-stu-id="458f1-170">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuración de Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="458f1-172">En una ventana del explorador web diferente, inicio de sesión tooyour Voyance inquilino como administrador.</span><span class="sxs-lookup"><span data-stu-id="458f1-172">In a different web browser window, sign-on tooyour Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="458f1-173">Vaya toohello la esquina superior derecha de la barra de navegación de Hola y haga clic en hello desplegable que dice "**Acme Universidad**".</span><span class="sxs-lookup"><span data-stu-id="458f1-173">Go toohello top right corner of hello navigation bar and click on hello drop-down that says "**Acme University**".</span></span>
    
    ![Configuración del inicio de sesión único en la aplicación Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="458f1-175">Haga clic en "**Configuración de administración**".</span><span class="sxs-lookup"><span data-stu-id="458f1-175">Click "**Admin Settings**".</span></span>

    ![Configuración del inicio de sesión único en la configuración de administrador de la aplicación](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="458f1-177">Haga clic en la pestaña "**Acceso de usuarios**".</span><span class="sxs-lookup"><span data-stu-id="458f1-177">Click "**User Access**" tab.</span></span>

    ![Configuración del inicio de sesión único en el acceso de usuarios de la aplicación](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="458f1-179">Haga clic en hello "**el SSO está deshabilitado**" botón tooconfigure Azure AD como un IdP mediante SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="458f1-179">Click hello "**SSO is disabled**" button tooconfigure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configuración del inicio de sesión único con el botón SSO deshabilitado en la aplicación](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="458f1-181">Vaya demasiado**SAML v2** sección y realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="458f1-181">Go too**SAML v2** section and perform below steps:</span></span>

    ![Configuración del inicio de sesión único en la configuración SAML v2 de la aplicación](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="458f1-183">a.</span><span class="sxs-lookup"><span data-stu-id="458f1-183">a.</span></span> <span data-ttu-id="458f1-184">Seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="458f1-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="458f1-185">b.</span><span class="sxs-lookup"><span data-stu-id="458f1-185">b.</span></span> <span data-ttu-id="458f1-186">Pegar **SAML Single Sign-On dirección URL del servicio**, que haya copiado desde Hola portal de Azure en hello **dirección URL de inicio de sesión IdP** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="458f1-186">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal Into hello **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="458f1-187">c.</span><span class="sxs-lookup"><span data-stu-id="458f1-187">c.</span></span> <span data-ttu-id="458f1-188">Abra el certificado codificado en Base64 descargado en el Bloc de notas, Hola copia contenido del mismo en el Portapapeles y, a continuación, péguelo toohello **IdP Cert** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="458f1-188">Open your downloaded Base64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="458f1-189">d.</span><span class="sxs-lookup"><span data-stu-id="458f1-189">d.</span></span> <span data-ttu-id="458f1-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="458f1-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="458f1-191">Ahora puede leer una versión concisa de estas instrucciones dentro de hello [portal de Azure](https://portal.azure.com), mientras que está configurando la aplicación hello!</span><span class="sxs-lookup"><span data-stu-id="458f1-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="458f1-192">Después de agregar esta aplicación de hello **Active Directory > aplicaciones empresariales** sección, simplemente haga clic en hello **Single Sign-On** Hola de pestaña y acceso incrustado documentación a través de hello ** Configuración** sección final Hola.</span><span class="sxs-lookup"><span data-stu-id="458f1-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="458f1-193">Puede leer más acerca de características de documentación de embedded Hola aquí: [Azure AD incrustado documentación]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="458f1-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="458f1-194">Creación de un usuario de prueba de Azure AD</span><span class="sxs-lookup"><span data-stu-id="458f1-194">Create an Azure AD test user</span></span>

<span data-ttu-id="458f1-195">objetivo de Hola de esta sección es un usuario de prueba en hello Azure portal llamado a Britta Simon toocreate.</span><span class="sxs-lookup"><span data-stu-id="458f1-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Creación de un usuario de prueba de Azure AD][100]

<span data-ttu-id="458f1-197">**toocreate un usuario de prueba en Azure AD, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="458f1-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="458f1-198">Hola **portal de Azure**, en Hola panel de navegación izquierdo, haga clic en **Azure Active Directory** icono.</span><span class="sxs-lookup"><span data-stu-id="458f1-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![botón de Hello Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="458f1-200">lista de hello toodisplay de usuarios, vaya demasiado**usuarios y grupos** y haga clic en **todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="458f1-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hola "Usuarios y grupos" y "Todos los usuarios" vínculos](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="458f1-202">Hola tooopen **usuario** cuadro de diálogo, haga clic en **agregar** en la parte superior de saludo del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="458f1-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![botón de agregar Hola](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="458f1-204">En hello **usuario** cuadro de diálogo, siga los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="458f1-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![cuadro de diálogo de usuario de Hola](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="458f1-206">a.</span><span class="sxs-lookup"><span data-stu-id="458f1-206">a.</span></span> <span data-ttu-id="458f1-207">Hola **nombre** cuadro de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="458f1-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="458f1-208">b.</span><span class="sxs-lookup"><span data-stu-id="458f1-208">b.</span></span> <span data-ttu-id="458f1-209">Hola **nombre de usuario** cuadro de texto, hello tipo **dirección de correo electrónico** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="458f1-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="458f1-210">c.</span><span class="sxs-lookup"><span data-stu-id="458f1-210">c.</span></span> <span data-ttu-id="458f1-211">Seleccione **Mostrar contraseña** y anote el valor de Hola de hello **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="458f1-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="458f1-212">d.</span><span class="sxs-lookup"><span data-stu-id="458f1-212">d.</span></span> <span data-ttu-id="458f1-213">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="458f1-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="458f1-214">Creación de un usuario de prueba de Voyance</span><span class="sxs-lookup"><span data-stu-id="458f1-214">Create a Voyance test user</span></span>

<span data-ttu-id="458f1-215">objetivo de Hola de esta sección es un usuario llamado a Britta Simon en Voyance toocreate.</span><span class="sxs-lookup"><span data-stu-id="458f1-215">hello objective of this section is toocreate a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="458f1-216">Voyance admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="458f1-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="458f1-217">No hay ningún elemento de acción para usted en esta sección.</span><span class="sxs-lookup"><span data-stu-id="458f1-217">There is no action item for you in this section.</span></span> <span data-ttu-id="458f1-218">Se crea un nuevo usuario durante un tooaccess intento Voyance si no existe todavía.</span><span class="sxs-lookup"><span data-stu-id="458f1-218">A new user is created during an attempt tooaccess Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="458f1-219">Si necesita un usuario toocreate manualmente, necesita toocontact [equipo de soporte técnico de Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="458f1-219">If you need toocreate a user manually, you need toocontact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="458f1-220">Asignar el usuario de prueba de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="458f1-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="458f1-221">En esta sección, se habilita Britta Simon toouse un inicio de sesión único Azure concediendo acceso tooVoyance.</span><span class="sxs-lookup"><span data-stu-id="458f1-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooVoyance.</span></span>

![Asigne el rol de usuario de Hola][200]

<span data-ttu-id="458f1-223">**tooassign Britta Simon tooVoyance, lleve a cabo Hola pasos:**</span><span class="sxs-lookup"><span data-stu-id="458f1-223">**tooassign Britta Simon tooVoyance, perform hello following steps:**</span></span>

1. <span data-ttu-id="458f1-224">Hola portal de Azure, abra la vista de aplicaciones de hello y, a continuación, navegue a vista de directorio toohello y vaya demasiado**aplicaciones empresariales** , a continuación, haga clic en **todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="458f1-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Asignar usuario][201] 

2. <span data-ttu-id="458f1-226">En la lista de aplicaciones de hello, seleccione **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="458f1-226">In hello applications list, select **Voyance**.</span></span>

    ![vínculo de Voyance Hello en la lista de aplicaciones de Hola](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="458f1-228">En el menú de Hola Hola izquierda, haga clic en **usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="458f1-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![vínculo de "Usuarios y grupos" Hello][202]

4. <span data-ttu-id="458f1-230">Haga clic en el botón **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="458f1-230">Click **Add** button.</span></span> <span data-ttu-id="458f1-231">Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="458f1-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![panel de agregar asignación de Hola][203]

5. <span data-ttu-id="458f1-233">En **usuarios y grupos** cuadro de diálogo, seleccione **Britta Simon** en la lista de usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="458f1-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="458f1-234">Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="458f1-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="458f1-235">Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="458f1-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="458f1-236">Prueba de inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="458f1-236">Test single sign-on</span></span>

<span data-ttu-id="458f1-237">En esta sección, comprobará su único inicio de sesión en configuración de Azure AD con hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="458f1-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="458f1-238">Al hacer clic en icono de Voyance Hola Hola Panel de acceso, deberá obtener automáticamente ha iniciado sesión tooyour Voyance aplicación.</span><span class="sxs-lookup"><span data-stu-id="458f1-238">When you click hello Voyance tile in hello Access Panel, you should get automatically signed-on tooyour Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="458f1-239">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="458f1-239">Additional resources</span></span>

* [<span data-ttu-id="458f1-240">Lista de tutoriales sobre cómo tooIntegrate aplicaciones de SaaS con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="458f1-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="458f1-241">¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="458f1-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

